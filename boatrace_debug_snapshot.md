# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-17T15:40:01.316220+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×66 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×70 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×66 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×20  [2026-08-17T15:20:28]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CIRCUIT_BREAKER_TRIP  ×70  [2026-08-17T15:05:37]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×105  [2026-08-17T15:05:37]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×35  [2026-08-17T15:05:37]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-08-17T15:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-08-17T15:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-08-17T15:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_BET_VOLUME_DROP  ×11  [2026-08-17T13:00:18]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×9  [2026-08-17T10:15:56]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-17T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=71<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-17T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S00: n=171<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-17T06:00:14]
- key: `DRIFT_BUCKET|drift ≤-30%: n=37 hit%=21.6% ROI=0.64 (コスト 10,600/回収 6,770)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-17T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=9 pred=0.1189 actual=0.1111 gap=+0.0078`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-17T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=12 pred=0.1827 actual=0.0833 gap=+0.0994`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-17T06:00:14]
- key: `DRIFT_BUCKET|drift ≥+30%: n=40 hit%=22.5% ROI=0.91 (コスト 11,000/回収 9,990)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-08-17T06:00:14]
- key: `ROI_STAT|S00: n=171 hit%=22.8% hit_CI[Bonf]=[14.9,33.2]% ROI=0.63 ROI_boot95=[0.44,0.87]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-17T06:00:14]
- key: `ROI_STAT|S01_NAKAANA1: n=176 hit%=21.6% hit_CI[Bonf]=[14.0,31.7]% ROI=0.69 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-17T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=176<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-17T06:00:14]
- key: `ROI_STAT|S02_TETSUBAN: n=71 hit%=50.7% hit_CI[Bonf]=[34.4,66.8]% ROI=0.80 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-08-17T06:00:14]
- key: `ORPHAN_SCAN|208 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 10.73MB / last modified 2026-08-17T15:39:38.699093+09:00

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
17 15:39:03,384 [INFO] run_cycle: === run_cycle 15:39:03 ===
2026-08-17 15:39:03,384 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-17 15:39:03,384 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-17 15:39:03,432 [INFO] predictor: Models loaded OK
2026-08-17 15:39:14,541 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=11&jcd=13&hd=20260817: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-08-17 15:39:24,854 [WARNING] scraper: beforeinfo parse failed: jcd=13 rno=11
2026-08-17 15:39:24,854 [WARNING] run_cycle: fetch None: 13/11
2026-08-17 15:39:28,327 [INFO] scraper: odds3t: 120/120 parsed
2026-08-17 15:39:29,394 [INFO] scraper: odds3f: 20/20 parsed
2026-08-17 15:39:30,467 [INFO] scraper: odds2t: 30/30 parsed
2026-08-17 15:39:30,468 [INFO] scraper: odds2f: 15/15 parsed
2026-08-17 15:39:31,536 [INFO] scraper: odds_win: 4/6 parsed
2026-08-17 15:39:31,536 [INFO] scraper: fetch_race 11/11: boats=6 odds=189/191
2026-08-17 15:39:31,540 [INFO] predictor: CALIBRATION_MODE=on
2026-08-17 15:39:31,540 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-08-17 15:39:31,543 [INFO] run_cycle: fetched 11/11 [scan]: 154 combos
2026-08-17 15:39:35,034 [INFO] scraper: odds3t: 120/120 parsed
2026-08-17 15:39:36,136 [INFO] scraper: odds3f: 19/20 parsed
2026-08-17 15:39:37,219 [INFO] scraper: odds2t: 29/30 parsed
2026-08-17 15:39:37,220 [INFO] scraper: odds2f: 15/15 parsed
2026-08-17 15:39:38,318 [INFO] scraper: odds_win: 3/6 parsed
2026-08-17 15:39:38,319 [INFO] scraper: fetch_race 20/2: boats=6 odds=186/191
2026-08-17 15:39:38,321 [INFO] predictor: CALIBRATION_MODE=on
2026-08-17 15:39:38,321 [INFO] predictor: combos: {'win': 3, '2t': 29, '3t': 120}
2026-08-17 15:39:38,325 [INFO] run_cycle: fetched 20/2 [scan]: 152 combos
2026-08-17 15:39:38,443 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 71
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 71
  }
]
```

## Phase別通知記録 (24h)
{'final': 28, 'result': 16, 'scan': 27}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 101
  FINAL_MISSING: 70
  CIRCUIT_BREAKER_TRIP: 66
  CIRCUIT_BREAKER_NO_ACTION: 51
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 9
  ANOMALY_BET_VOLUME_DROP: 2
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 43 | 9 | 12,900 | 6,180 | -6,720 | 0.479 |
| S01_NAKAANA1 | 48 | 11 | 9,600 | 7,180 | -2,420 | 0.748 |
| S02_TETSUBAN | 21 | 8 | 4,200 | 2,280 | -1,920 | 0.543 |

## 直近アラート (24h・新しい順)
```
[15:38:44] CIRCUIT_BREAKER_TRIP: {"cost": 12900, "kind": "CIRCUIT_BREAKER_TRIP", "n": 43, "payout": 6180, "roi_7d": 0.479, "sid": "S00"}
[15:31:59] FINAL_MISSING: {"deadline": "2026-08-17T11:59:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081714081159", "sid": "S00"}
[15:31:59] FINAL_MISSING: {"deadline": "2026-08-17T13:00:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081710101300", "sid": "S00"}
[15:20:28] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": -0.23, "baseline_mean": 0.72, "baseline_stdev": 0.096, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.95, "today_scan_count": 20, "z_score": 2.39}
[15:05:36] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[15:05:36] CIRCUIT_BREAKER_TRIP: {"cost": 4200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 21, "payout": 2280, "roi_7d": 0.543, "sid": "S02_TETSUBAN"}
[15:05:36] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[15:05:36] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[15:05:36] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[15:04:27] CIRCUIT_BREAKER_TRIP: {"cost": 4000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 20, "payout": 2280, "roi_7d": 0.57, "sid": "S02_TETSUBAN"}
```

## 本日残レース: 60件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 108件 締切済
- 通知発射: scan=20 nid / final=22 nid / result=12 nid
- predictions: 13 / うち結果DB記録済: 13
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 2件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 058R | win | 1 | 0.5253 | 2.4 | 1.26 | 200 | scan=- drift=- | 15:05:19 |
| S00 | 058R | win | 1 | 0.5253 | 18.5 | 9.72 | 300 | scan=42.0 drift=-56.0% | 15:04:19 |
| S02_TETSUBAN | 057R | win | 1 | 0.5663 | 2.4 | 1.36 | 200 | scan=- drift=- | 14:33:18 |
| S02_TETSUBAN | 139R | win | 1 | 0.5476 | 2.4 | 1.31 | 200 | scan=- drift=- | 14:30:20 |
| S01_NAKAANA1 | 178R | win | 1 | 0.3177 | 3.9 | 1.24 | 200 | scan=3.8 drift=+2.6% | 14:11:19 |
| S00 | 118R | win | 1 | 0.4092 | 7.5 | 3.07 | 300 | scan=8.2 drift=-8.5% | 14:04:18 |
| S00 | 177R | win | 1 | 0.2173 | 16.8 | 3.65 | 300 | scan=11.2 drift=+50.0% | 13:26:18 |
| S00 | 026R | win | 1 | 0.3177 | 5.0 | 1.59 | 300 | scan=7.5 drift=-33.3% | 13:11:18 |
| S00 | 1410R | win | 1 | 0.4111 | 5.7 | 2.34 | 300 | scan=5.6 drift=+1.8% | 13:02:26 |
| S01_NAKAANA1 | 096R | win | 1 | 0.4111 | 3.6 | 1.48 | 200 | scan=3.4 drift=+5.9% | 12:47:43 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 69 | +4.2% | -62.9% | +207.5% | 18 | 9 | 35 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 483.8s |
| **Latency** (scan→final max) | 602.3s |
| **Traffic** (notifications 24h) | 71 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 2,100円 used |
| **Saturation** (S01_NAKAANA1) | 600円 used |
| **Saturation** (S02_TETSUBAN) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 415 | 0.4653 | 0.2723 | +0.1930 | 🟡+42% | 0.2368 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 168 | 0.4156 | 0.2262 | 0.2188 | 🔴-0.25 | 0.631 |
| S01_NAKAANA1 | win | 174 | 0.4860 | 0.2241 | 0.2508 | 🔴-0.44 | 0.726 |
| S02_TETSUBAN | win | 73 | 0.5303 | 0.4932 | 0.2444 | ✅+0.02 | 0.777 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 9 | 0.1189 | 0.1111 | ✅+0.0078 |
| 0.15-0.20 | 12 | 0.1827 | 0.0833 | 🔴+0.0994 |
| 0.20-0.30 | 8 | 0.2246 | 0.3750 | 🔴-0.1504 |
| 0.30-0.50 | 158 | 0.4138 | 0.2342 | 🔴+0.1796 |
| 0.50+ | 226 | 0.5420 | 0.3142 | 🔴+0.2278 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 111 | 0.765 |
| win | <5.0 | ✅learned | 191 | 0.734 |
| win | <10.0 | ✅learned | 96 | 0.446 |
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
_auto-generated by claude_snapshot.py at 2026-08-17T15:40:01.316220+09:00_