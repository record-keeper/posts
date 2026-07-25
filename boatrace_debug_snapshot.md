# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-07-25T13:30:01.518109+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×97 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×3 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-07-25T13:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-07-25T13:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×54  [2026-07-25T13:03:15]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×27  [2026-07-25T13:03:15]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_DROP  ×21  [2026-07-25T13:00:51]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🔴 CIRCUIT_BREAKER_TRIP  ×10  [2026-07-25T12:05:22]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×12  [2026-07-25T10:29:42]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×20  [2026-07-25T10:23:20]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-07-25T10:00:02]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-25T06:00:06]
- key: `INSUFFICIENT_SAMPLE|S00: n=183<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-25T06:00:06]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=76<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-25T06:00:06]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=166<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-25T06:00:06]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=34 pred=0.3245 actual=0.0882 gap=+0.2362`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-25T06:00:06]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=44 hit%=31.8% ROI=0.88 (コスト 10,700/回収 9,390)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-25T06:00:06]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1267 actual=0.1667 gap=-0.0400`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-25T06:00:06]
- key: `ROI_STAT|S00: n=183 hit%=28.4% hit_CI[Bonf]=[19.9,38.8]% ROI=0.76 ROI_boot95=[0.56,0.99]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-25T06:00:06]
- key: `ROI_STAT|S01_NAKAANA1: n=166 hit%=27.7% hit_CI[Bonf]=[18.9,38.6]% ROI=0.77 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-25T06:00:06]
- key: `ROI_STAT|S02_TETSUBAN: n=76 hit%=50.0% hit_CI[Bonf]=[34.3,65.7]% ROI=0.98 ROI_boot95=[0.7`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-07-25T06:00:06]
- key: `ORPHAN_SCAN|180 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-25T06:00:06]
- key: `DRIFT_BUCKET|drift ≤-30%: n=34 hit%=29.4% ROI=0.61 (コスト 10,000/回収 6,090)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 8.7MB / last modified 2026-07-25T13:30:04.664219+09:00

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
hd=20260725: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-07-25 13:29:26,434 [INFO] scraper: odds3t: 120/120 parsed
2026-07-25 13:29:27,514 [INFO] scraper: odds3f: 20/20 parsed
2026-07-25 13:29:28,619 [INFO] scraper: odds2t: 30/30 parsed
2026-07-25 13:29:28,620 [INFO] scraper: odds2f: 15/15 parsed
2026-07-25 13:29:29,690 [INFO] scraper: odds_win: 4/6 parsed
2026-07-25 13:29:29,690 [INFO] scraper: fetch_race 14/11: boats=6 odds=189/191
2026-07-25 13:29:29,701 [INFO] predictor: CALIBRATION_MODE=on
2026-07-25 13:29:29,702 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-07-25 13:29:29,709 [INFO] run_cycle: fetched 14/11 [scan]: 154 combos
2026-07-25 13:29:33,227 [INFO] scraper: odds3t: 120/120 parsed
2026-07-25 13:29:34,321 [INFO] scraper: odds3f: 20/20 parsed
2026-07-25 13:29:35,398 [INFO] scraper: odds2t: 30/30 parsed
2026-07-25 13:29:35,399 [INFO] scraper: odds2f: 14/15 parsed
2026-07-25 13:29:36,465 [INFO] scraper: odds_win: 6/6 parsed
2026-07-25 13:29:36,465 [INFO] scraper: fetch_race 06/5: boats=6 odds=190/191
2026-07-25 13:29:36,467 [INFO] predictor: CALIBRATION_MODE=on
2026-07-25 13:29:36,467 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-07-25 13:29:36,471 [INFO] run_cycle: fetched 06/5 [scan]: 156 combos
2026-07-25 13:29:39,885 [INFO] scraper: odds3t: 120/120 parsed
2026-07-25 13:29:40,965 [INFO] scraper: odds3f: 20/20 parsed
2026-07-25 13:29:42,039 [INFO] scraper: odds2t: 26/30 parsed
2026-07-25 13:29:42,040 [INFO] scraper: odds2f: 14/15 parsed
2026-07-25 13:29:43,109 [INFO] scraper: odds_win: 3/6 parsed
2026-07-25 13:29:43,109 [INFO] scraper: fetch_race 17/6: boats=6 odds=183/191
2026-07-25 13:29:43,111 [INFO] predictor: CALIBRATION_MODE=on
2026-07-25 13:29:43,111 [INFO] predictor: combos: {'win': 3, '2t': 26, '3t': 120}
2026-07-25 13:29:43,115 [INFO] run_cycle: fetched 17/6 [scan]: 149 combos
2026-07-25 13:29:43,226 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 57
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 57
  }
]
```

## Phase別通知記録 (24h)
{'final': 23, 'result': 11, 'scan': 23}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 145
  FINAL_MISSING: 97
  CIRCUIT_BREAKER_NO_ACTION: 34
  STRATEGY_CI_FAIL: 17
  CIRCUIT_BREAKER_TRIP: 3
  ANOMALY_BET_VOLUME_DROP: 2
  ANOMALY_SCAN_FINAL_RATIO: 2
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 47 | 11 | 14,100 | 9,990 | -4,110 | 0.709 |
| S01_NAKAANA1 | 38 | 7 | 7,600 | 5,460 | -2,140 | 0.718 |
| S02_TETSUBAN | 15 | 9 | 3,000 | 3,220 | +220 | 1.073 |

## 直近アラート (24h・新しい順)
```
[13:05:20] FINAL_MISSING: {"deadline": "2026-07-25T12:35:00+09:00", "kind": "FINAL_MISSING", "nid": "2026072503041235", "sid": "S00"}
[13:03:15] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[13:03:15] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[13:03:15] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[13:00:51] ANOMALY_BET_VOLUME_DROP: {"baseline_mean": 8.9, "baseline_n_days": 7, "baseline_stdev": 3.2, "hour": 13, "kind": "ANOMALY_BET_VOLUME_DROP", "today_so_far": 2, "z_score": -2.15}
[12:44:28] FINAL_MISSING: {"deadline": "2026-07-25T09:12:00+09:00", "kind": "FINAL_MISSING", "nid": "2026072514020912", "sid": "S00"}
[12:05:22] CIRCUIT_BREAKER_TRIP: {"cost": 8000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 40, "payout": 5460, "roi_7d": 0.682, "sid": "S01_NAKAANA1"}
[12:02:26] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[12:02:26] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[12:02:26] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
```

## 本日残レース: 110件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 180件 登録 / 70件 締切済
- 通知発射: scan=8 nid / final=8 nid / result=2 nid
- predictions: 3 / うち結果DB記録済: 2
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 3件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 044R | win | 1 | 0.4111 | 3.2 | 1.32 | 200 | scan=- drift=- | 13:21:17 |
| S01_NAKAANA1 | 033R | win | 1 | 0.4111 | 3.5 | 1.44 | 200 | scan=- drift=- | 12:05:19 |
| S00 | 218R | win | 1 | 0.1720 | 5.1 | 0.88 | 300 | scan=- drift=- | 11:40:20 |
| S00 | 0111R | win | 1 | 0.5735 | 6.5 | 3.73 | 300 | scan=23.0 drift=-71.7% | 19:59:19 |
| S01_NAKAANA1 | 019R | win | 1 | 0.3177 | 3.4 | 1.08 | 200 | scan=- drift=- | 19:06:18 |
| S00 | 015R | win | 1 | 0.0923 | 5.7 | 0.53 | 300 | scan=- drift=- | 17:21:30 |
| S00 | 153R | win | 1 | 0.1957 | 14.2 | 2.78 | 300 | scan=- drift=- | 16:31:30 |
| S02_TETSUBAN | 1310R | win | 1 | 0.5039 | 2.6 | 1.31 | 200 | scan=- drift=- | 15:08:30 |
| S00 | 225R | win | 1 | 0.4111 | 4.5 | 1.85 | 300 | scan=- drift=- | 14:15:43 |
| S01_NAKAANA1 | 028R | win | 1 | 0.5891 | 3.8 | 2.24 | 200 | scan=4.0 drift=-5.0% | 14:13:18 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 46 | +24.7% | -83.7% | +628.9% | 18 | 9 | 36 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 479.5s |
| **Latency** (scan→final max) | 663.8s |
| **Traffic** (notifications 24h) | 57 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 300円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 422 | 0.4649 | 0.3223 | +0.1426 | 🟡+31% | 0.2338 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 180 | 0.4210 | 0.2889 | 0.2221 | 🔴-0.08 | 0.777 |
| S01_NAKAANA1 | win | 166 | 0.4774 | 0.2771 | 0.2376 | 🔴-0.19 | 0.767 |
| S02_TETSUBAN | win | 76 | 0.5413 | 0.5000 | 0.2530 | 🔴-0.01 | 0.984 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1267 | 0.1667 | ✅-0.0400 |
| 0.15-0.20 | 9 | 0.1804 | 0.3333 | 🔴-0.1530 |
| 0.20-0.30 | 13 | 0.2273 | 0.3077 | 🔴-0.0804 |
| 0.30-0.50 | 167 | 0.4169 | 0.2814 | 🔴+0.1355 |
| 0.50+ | 223 | 0.5420 | 0.3632 | 🔴+0.1788 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 84 | 0.805 |
| win | <5.0 | ✅learned | 152 | 0.725 |
| win | <10.0 | ✅learned | 80 | 0.46 |
| win | <20.0 | ✅learned | 26 | 0.216 |
| win | <50.0 | ⚠️fallback | 6 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-07-25T13:30:01.518109+09:00_