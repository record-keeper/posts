# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-19T19:50:02.073050+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×21 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×49 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×21 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-19T19:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-19T19:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CIRCUIT_BREAKER_TRIP  ×43  [2026-08-19T19:07:33]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×86  [2026-08-19T19:07:33]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×43  [2026-08-19T19:07:33]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_DROP  ×10  [2026-08-19T15:01:05]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×23  [2026-08-19T13:21:00]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×10  [2026-08-19T10:24:45]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-19T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S00: n=164<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-19T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=75<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-08-19T06:00:11]
- key: `ORPHAN_SCAN|194 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-19T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=9 pred=0.1189 actual=0.1111 gap=+0.0078`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-19T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=172<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-19T06:00:11]
- key: `DRIFT_BUCKET|drift ≤-30%: n=36 hit%=22.2% ROI=0.65 (コスト 10,400/回収 6,770)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-19T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=8 pred=0.2246 actual=0.3750 gap=-0.1504`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-19T06:00:11]
- key: `ROI_STAT|S00: n=164 hit%=24.4% hit_CI[Bonf]=[16.1,35.2]% ROI=0.77 ROI_boot95=[0.51,1.07]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-19T06:00:11]
- key: `ROI_STAT|S01_NAKAANA1: n=172 hit%=23.3% hit_CI[Bonf]=[15.3,33.7]% ROI=0.82 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-19T06:00:11]
- key: `ROI_STAT|S02_TETSUBAN: n=75 hit%=46.7% hit_CI[Bonf]=[31.2,62.8]% ROI=0.72 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-19T06:00:11]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=31 hit%=35.5% ROI=1.17 (コスト 7,300/回収 8,510)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-19T06:00:11]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=87 hit%=27.6% ROI=0.89 (コスト 20,200/回収 17,890)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 10.93MB / last modified 2026-08-19T19:49:05.874603+09:00

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
FO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-19 19:47:04,377 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-19 19:47:04,426 [INFO] predictor: Models loaded OK
2026-08-19 19:47:04,534 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-19 19:48:04,164 [INFO] run_cycle: === run_cycle 19:48:04 ===
2026-08-19 19:48:04,164 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-19 19:48:04,164 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-19 19:48:04,195 [INFO] predictor: Models loaded OK
2026-08-19 19:48:15,280 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=11&jcd=15&hd=20260819: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-08-19 19:48:26,813 [INFO] scraper: odds3t: 120/120 parsed
2026-08-19 19:48:27,887 [INFO] scraper: odds3f: 20/20 parsed
2026-08-19 19:48:28,994 [INFO] scraper: odds2t: 30/30 parsed
2026-08-19 19:48:28,995 [INFO] scraper: odds2f: 15/15 parsed
2026-08-19 19:48:30,100 [INFO] scraper: odds_win: 6/6 parsed
2026-08-19 19:48:30,100 [INFO] scraper: fetch_race 15/11: boats=6 odds=191/191
2026-08-19 19:48:30,103 [INFO] predictor: CALIBRATION_MODE=on
2026-08-19 19:48:30,103 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-08-19 19:48:30,107 [INFO] run_cycle: fetched 15/11 [scan]: 156 combos
2026-08-19 19:48:30,340 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-19 19:49:04,632 [INFO] run_cycle: === run_cycle 19:49:04 ===
2026-08-19 19:49:04,632 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-19 19:49:04,632 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-19 19:49:04,666 [INFO] predictor: Models loaded OK
2026-08-19 19:49:04,767 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 68
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 68
  }
]
```

## Phase別通知記録 (24h)
{'final': 26, 'result': 15, 'scan': 27}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 49
  ANOMALY_SCRAPER_FAILURE_BURST: 47
  CIRCUIT_BREAKER_NO_ACTION: 38
  CIRCUIT_BREAKER_TRIP: 21
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 3
  ANOMALY_BET_VOLUME_DROP: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 46 | 15 | 13,800 | 17,400 | +3,600 | 1.261 |
| S01_NAKAANA1 | 48 | 13 | 9,600 | 11,280 | +1,680 | 1.175 |
| S02_TETSUBAN | 23 | 5 | 4,600 | 1,580 | -3,020 | 0.343 |

## 直近アラート (24h・新しい順)
```
[19:45:25] FINAL_MISSING: {"deadline": "2026-08-19T15:13:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081911101513", "sid": "S00"}
[19:39:04] FINAL_MISSING: {"deadline": "2026-08-19T16:08:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081915031608", "sid": "S00"}
[19:37:20] FINAL_MISSING: {"deadline": "2026-08-19T14:04:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081905061404", "sid": "S00"}
[19:36:04] CIRCUIT_BREAKER_TRIP: {"cost": 4600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 23, "payout": 1580, "roi_7d": 0.343, "sid": "S02_TETSUBAN"}
[19:25:05] FINAL_MISSING: {"deadline": "2026-08-19T15:53:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081919021553", "sid": "S00"}
[19:25:05] FINAL_MISSING: {"deadline": "2026-08-19T17:55:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081915071755", "sid": "S00"}
[19:07:31] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[19:07:31] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[19:07:31] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[19:02:21] FINAL_MISSING: {"deadline": "2026-08-19T11:27:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081914071127", "sid": "S00"}
```

## 本日残レース: 6件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 138件 締切済
- 通知発射: scan=23 nid / final=23 nid / result=13 nid
- predictions: 15 / うち結果DB記録済: 15
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 6件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 206R | win | 1 | 0.5174 | 2.2 | 1.14 | 200 | scan=- drift=- | 17:34:19 |
| S02_TETSUBAN | 204R | win | 1 | 0.5123 | 2.0 | 1.02 | 200 | scan=2.0 drift=+0.0% | 16:37:20 |
| S01_NAKAANA1 | 193R | win | 1 | 0.5174 | 4.5 | 2.33 | 200 | scan=4.5 drift=+0.0% | 16:18:21 |
| S00 | 193R | win | 1 | 0.5174 | 4.5 | 2.33 | 300 | scan=4.5 drift=+0.0% | 16:18:18 |
| S02_TETSUBAN | 203R | win | 1 | 0.5334 | 2.0 | 1.07 | 200 | scan=- drift=- | 16:09:19 |
| S00 | 152R | win | 1 | 0.1543 | 6.3 | 0.97 | 300 | scan=4.5 drift=+40.0% | 15:41:19 |
| S02_TETSUBAN | 1110R | win | 1 | 0.5123 | 2.6 | 1.33 | 200 | scan=2.1 drift=+23.8% | 15:11:20 |
| S01_NAKAANA1 | 056R | win | 1 | 0.5735 | 4.2 | 2.41 | 200 | scan=- drift=- | 14:02:19 |
| S01_NAKAANA1 | 137R | win | 1 | 0.5331 | 3.8 | 2.03 | 200 | scan=3.0 drift=+26.7% | 13:25:21 |
| S00 | 116R | win | 1 | 0.5476 | 7.5 | 4.11 | 300 | scan=5.2 drift=+44.2% | 13:05:19 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 72 | +6.9% | -62.9% | +207.5% | 13 | 6 | 32 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 475.8s |
| **Latency** (scan→final max) | 612.7s |
| **Traffic** (notifications 24h) | 68 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,800円 used |
| **Saturation** (S01_NAKAANA1) | 1,000円 used |
| **Saturation** (S02_TETSUBAN) | 800円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 416 | 0.4663 | 0.2837 | +0.1827 | 🟡+39% | 0.2392 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 165 | 0.4139 | 0.2545 | 0.2212 | 🔴-0.17 | 0.791 |
| S01_NAKAANA1 | win | 173 | 0.4875 | 0.2370 | 0.2525 | 🔴-0.40 | 0.829 |
| S02_TETSUBAN | win | 78 | 0.5303 | 0.4487 | 0.2481 | 🔴-0.00 | 0.706 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 9 | 0.1189 | 0.1111 | ✅+0.0078 |
| 0.15-0.20 | 11 | 0.1804 | 0.0909 | 🔴+0.0895 |
| 0.20-0.30 | 10 | 0.2255 | 0.3000 | 🔴-0.0745 |
| 0.30-0.50 | 154 | 0.4144 | 0.2532 | 🔴+0.1612 |
| 0.50+ | 230 | 0.5422 | 0.3217 | 🔴+0.2204 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 113 | 0.769 |
| win | <5.0 | ✅learned | 200 | 0.757 |
| win | <10.0 | ✅learned | 100 | 0.457 |
| win | <20.0 | ✅learned | 30 | 0.227 |
| win | <50.0 | ⚠️fallback | 7 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-08-19T19:50:02.073050+09:00_