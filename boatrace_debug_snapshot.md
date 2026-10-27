# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-27T14:00:01.833206+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×25 (24h) → ログ/DB確認

### 検出された問題
- 🔴 CIRCUIT_BREAKER_TRIP×25 (24h)
- 🟡 FINAL_MISSING×19 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 SNAPSHOT_STALE×10 (24h)
- 🔴 SEND_WITHOUT_DBREC×8 (24h)
- 🟡 LARGE_ODDS_DRIFT×3 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-10-27T14:00:07]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-10-27T14:00:07]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CIRCUIT_BREAKER_TRIP  ×56  [2026-10-27T13:03:34]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×112  [2026-10-27T13:03:34]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×56  [2026-10-27T13:03:34]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×11  [2026-10-27T11:49:29]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-27T06:00:22]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=73<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-10-27T06:00:22]
- key: `ORPHAN_SCAN|161 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-27T06:00:22]
- key: `INSUFFICIENT_SAMPLE|S00: n=189<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-27T06:00:22]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=193<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-27T06:00:22]
- key: `DRIFT_BUCKET|drift ≥+30%: n=50 hit%=26.0% ROI=0.83 (コスト 12,900/回収 10,660)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-27T06:00:22]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=45 hit%=31.1% ROI=0.60 (コスト 11,000/回収 6,590)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-27T06:00:22]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=9 pred=0.2288 actual=0.2222 gap=+0.0066`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-27T06:00:22]
- key: `ROI_STAT|S00: n=189 hit%=30.2% hit_CI[Bonf]=[21.5,40.5]% ROI=0.82 ROI_boot95=[0.62,1.04]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-27T06:00:22]
- key: `ROI_STAT|S01_NAKAANA1: n=193 hit%=33.7% hit_CI[Bonf]=[24.7,44.0]% ROI=0.89 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-27T06:00:22]
- key: `ROI_STAT|S02_TETSUBAN: n=73 hit%=52.1% hit_CI[Bonf]=[35.9,67.8]% ROI=0.90 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-27T06:00:22]
- key: `DRIFT_BUCKET|drift ≤-30%: n=27 hit%=44.4% ROI=1.24 (コスト 7,800/回収 9,660)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-27T06:00:22]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=86 hit%=41.9% ROI=1.13 (コスト 19,500/回収 22,060)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-27T06:00:22]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=66 hit%=31.8% ROI=0.85 (コスト 15,800/回収 13,360)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-27T06:00:22]
- key: `CALIBRATION_LIVE|bt=win: n=455 pred=0.4794 actual=0.3516 error=+0.1277 (+27%) brier=0.2393 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 16.95MB / last modified 2026-10-27T13:59:40.856521+09:00

### データファイル存在確認
| file | exists | md5 | size |
|---|---|---|---|
| lgbm_model_top1.txt | True | `5b55d55bdb59df95ccfd1745d4e9b469` | 769682 |
| lgbm_model_top3.txt | True | `d5fd8d8393fd859ed913813abbf60084` | 969111 |
| calibration_v7.json | True | `1c04ab3c1a1f074da889e6f5f06adbf3` | 1450 |
| pl_corr_v8_final.json | True | `8727224dfcc3d7548845e2e41caef7be` | 1209 |

### crontab
```
# boatrace_v2 - managed by めう/Claude
SHELL=/bin/bash
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# 1分毎: 統合サイクル (run_cycle.py, flock で並行実行防止)
* 8-23 * * * cd /opt/boatrace_v2 && flock -n /var/lock/run_cycle.lock /opt/boatrace/venv/bin/python3 run_cycle.py >> logs/run_cycle.log 2>&1

# 10分毎: pending alert flush
*/10 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 dispatch_pending.py >> logs/dispatch.log 2>&1

# 10分毎: snapshot 生成 + GitHub 同期 (Claude 次セッション用)
*/10 * * * * cd /opt/boatrace_v2 && bash sync_snapshot_to_github.sh >> logs/sync_snapshot.log 2>&1

# 5分毎: 結果取得
*/5 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 record_results.py >> logs/results.log 2>&1

# 30分毎: health check
*/30 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 health.py >> logs/health.log 2>&1

# 6時: 日次総合検査
0 6 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 verify_all.py >> logs/verify_all.log 2>&1

# 0時: 日次集計
5 0 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 daily_summary.py >> logs/daily.log 2>&1
0 3 * * * find /opt -maxdepth 1 -name "boatrace_v2.bak_*" -mtime +7 -exec rm -rf {} \; # backup cleanup

# 30分毎: コード/DB a
```

### 直近 run_cycle ログ (末尾)
```
204)
2026-10-27 13:58:35,304 [INFO] run_cycle: SCAN S00 児島8R SS
2026-10-27 13:58:35,460 [INFO] run_cycle: run_cycle done: 1 notifications
2026-10-27 13:59:05,088 [INFO] run_cycle: === run_cycle 13:59:05 ===
2026-10-27 13:59:05,088 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-27 13:59:05,088 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-27 13:59:05,157 [INFO] predictor: Models loaded OK
2026-10-27 13:59:16,212 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=8&jcd=03&hd=20261027: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-10-27 13:59:27,616 [INFO] scraper: odds3t: 120/120 parsed
2026-10-27 13:59:28,686 [INFO] scraper: odds3f: 20/20 parsed
2026-10-27 13:59:29,792 [INFO] scraper: odds2t: 30/30 parsed
2026-10-27 13:59:29,793 [INFO] scraper: odds2f: 15/15 parsed
2026-10-27 13:59:30,929 [INFO] scraper: odds_win: 3/6 parsed
2026-10-27 13:59:30,929 [INFO] scraper: fetch_race 03/8: boats=6 odds=188/191
2026-10-27 13:59:30,932 [INFO] predictor: CALIBRATION_MODE=on
2026-10-27 13:59:30,932 [INFO] predictor: combos: {'win': 3, '2t': 30, '3t': 120}
2026-10-27 13:59:30,936 [INFO] run_cycle: fetched 03/8 [final]: 153 combos
2026-10-27 13:59:34,541 [INFO] scraper: odds3t: 120/120 parsed
2026-10-27 13:59:35,638 [INFO] scraper: odds3f: 20/20 parsed
2026-10-27 13:59:36,774 [INFO] scraper: odds2t: 30/30 parsed
2026-10-27 13:59:36,775 [INFO] scraper: odds2f: 15/15 parsed
2026-10-27 13:59:37,844 [INFO] scraper: odds_win: 6/6 parsed
2026-10-27 13:59:37,844 [INFO] scraper: fetch_race 13/8: boats=6 odds=191/191
2026-10-27 13:59:38,675 [INFO] predictor: CALIBRATION_MODE=on
2026-10-27 13:59:38,676 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-10-27 13:59:38,680 [INFO] run_cycle: fetched 13/8 [final]: 156 combos
2026-10-27 13:59:39,152 [INFO] run_cycle: run_cycle done: 0 notifications

```

## 戦略有効/無効一覧
| id | trust | bt | ev_th | pmin | enabled |
|---|---|---|---|---|---|
| S00 | S | win | 4.0 | 0.0 | True |
| S01_NAKAANA1 | A | win | 1.5 | 0.0 | True |
| S02_TETSUBAN | A | win | 1.0 | 0.0 | True |
| S03_NAKAANA4 | B | win | 1.0 | 0.0 | False |
| S04_SELL_3T | B | 3t | 1.0 | 0.0 | False |
| S05_2T_MANKEN | B | 2t | 1.0 | 0.0 | False |
| S06_2F_AXIS1 | B | 2f | 1.0 | 0.0 | False |
| S07_2T_HONMEI | B | 2t | 1.0 | 0.0 | False |

## Webhook送信 (24h)
```
[
  {
    "target": "mirror",
    "ok": 1,
    "c": 83
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 84
  }
]
```

## Phase別通知記録 (24h)
{'final': 35, 'result': 18, 'scan': 30}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 105
  CIRCUIT_BREAKER_NO_ACTION: 34
  CIRCUIT_BREAKER_TRIP: 25
  ANOMALY_SCAN_FINAL_RATIO: 21
  FINAL_MISSING: 19
  STRATEGY_CI_FAIL: 17
  SNAPSHOT_STALE: 10
  SEND_WITHOUT_DBREC: 8
  LARGE_ODDS_DRIFT: 3
  ANOMALY_BET_VOLUME_SPIKE: 2
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 46 | 14 | 13,800 | 11,100 | -2,700 | 0.804 |
| S01_NAKAANA1 | 53 | 12 | 10,600 | 5,700 | -4,900 | 0.538 |
| S02_TETSUBAN | 13 | 7 | 2,600 | 4,840 | +2,240 | 1.862 |

## 直近アラート (24h・新しい順)
```
[13:42:32] CIRCUIT_BREAKER_TRIP: {"cost": 10600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 53, "payout": 5700, "roi_7d": 0.538, "sid": "S01_NAKAANA1"}
[13:32:38] CIRCUIT_BREAKER_TRIP: {"cost": 10600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 53, "payout": 4880, "roi_7d": 0.46, "sid": "S01_NAKAANA1"}
[13:11:42] CIRCUIT_BREAKER_TRIP: {"cost": 10400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 52, "payout": 4880, "roi_7d": 0.469, "sid": "S01_NAKAANA1"}
[13:08:31] CIRCUIT_BREAKER_TRIP: {"cost": 10200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 51, "payout": 4880, "roi_7d": 0.478, "sid": "S01_NAKAANA1"}
[13:01:40] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[13:01:40] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[13:01:40] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[12:23:27] CIRCUIT_BREAKER_TRIP: {"cost": 10000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 50, "payout": 4880, "roi_7d": 0.488, "sid": "S01_NAKAANA1"}
[12:01:35] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[12:01:35] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
```

## 本日残レース: 88件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 80件 締切済
- 通知発射: scan=16 nid / final=18 nid / result=11 nid
- predictions: 13 / うち結果DB記録済: 11
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 1件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 057R | win | 1 | 0.5891 | 2.3 | 1.35 | 200 | scan=2.3 drift=+0.0% | 13:34:21 |
| S01_NAKAANA1 | 037R | win | 1 | 0.3177 | 3.5 | 1.11 | 200 | scan=3.0 drift=+16.7% | 13:32:21 |
| S01_NAKAANA1 | 046R | win | 1 | 0.5123 | 4.8 | 2.46 | 200 | scan=- drift=- | 13:11:30 |
| S01_NAKAANA1 | 166R | win | 1 | 0.5123 | 3.7 | 1.90 | 200 | scan=- drift=- | 13:08:20 |
| S00 | 223R | win | 1 | 0.4111 | 22.5 | 9.25 | 300 | scan=- drift=- | 12:01:20 |
| S02_TETSUBAN | 134R | win | 1 | 0.4936 | 2.2 | 1.09 | 200 | scan=- drift=- | 11:55:20 |
| S00 | 033R | win | 1 | 0.2290 | 7.5 | 1.72 | 300 | scan=- drift=- | 11:49:19 |
| S02_TETSUBAN | 163R | win | 1 | 0.5174 | 2.0 | 1.03 | 200 | scan=2.6 drift=-23.1% | 11:42:31 |
| S00 | 053R | win | 1 | 0.4111 | 10.8 | 4.44 | 300 | scan=7.1 drift=+52.1% | 11:35:24 |
| S00 | 107R | win | 1 | 0.4989 | 8.0 | 3.99 | 300 | scan=8.2 drift=-2.4% | 11:32:19 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 55 | +7.2% | -77.4% | +111.7% | 15 | 4 | 36 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 423.4s |
| **Latency** (scan→final max) | 661.2s |
| **Traffic** (notifications 24h) | 83 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,500円 used |
| **Saturation** (S01_NAKAANA1) | 1,000円 used |
| **Saturation** (S02_TETSUBAN) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 459 | 0.4789 | 0.3508 | +0.1281 | 🟡+27% | 0.2392 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 192 | 0.4435 | 0.3021 | 0.2342 | 🔴-0.11 | 0.824 |
| S01_NAKAANA1 | win | 195 | 0.4892 | 0.3385 | 0.2384 | 🔴-0.06 | 0.925 |
| S02_TETSUBAN | win | 72 | 0.5450 | 0.5139 | 0.2546 | 🔴-0.02 | 1.079 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 9 | 0.1865 | 0.0000 | 🔴+0.1865 |
| 0.20-0.30 | 10 | 0.2288 | 0.2000 | ✅+0.0288 |
| 0.30-0.50 | 161 | 0.4139 | 0.3106 | 🔴+0.1033 |
| 0.50+ | 274 | 0.5425 | 0.3905 | 🔴+0.1520 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 196 | 0.811 |
| win | <5.0 | ✅learned | 354 | 0.742 |
| win | <10.0 | ✅learned | 155 | 0.451 |
| win | <20.0 | ✅learned | 46 | 0.252 |
| win | <50.0 | ⚠️fallback | 8 | 0.1 |
| win | ∞ | ⚠️fallback | 0 | 0.1 |
| 2t | <10.0 | ⚠️fallback | 0 | 0.5 |
| 2t | <30.0 | ⚠️fallback | 0 | 0.35 |
| 2t | ∞ | ⚠️fallback | 0 | 0.25 |
| 3t | <10.0 | ⚠️fallback | 1 | 0.4 |
| 3t | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3t | <200.0 | ⚠️fallback | 0 | 0.3 |
| 3t | ∞ | ⚠️fallback | 0 | 0.2 |
| 2f | <10.0 | ⚠️fallback | 0 | 0.45 |
| 2f | ∞ | ⚠️fallback | 0 | 0.3 |
| 3f | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3f | ∞ | ⚠️fallback | 0 | 0.25 |

---
_auto-generated by claude_snapshot.py at 2026-10-27T14:00:01.833206+09:00_